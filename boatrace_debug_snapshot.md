# ClaudeDebug スナップショット

## 🟡 現状: YELLOW

**生成**: 2026-04-23T02:10:01.927811+09:00

### 次に取るべきアクション
> YELLOW監視: FINAL_MISSING×123 (24h)

### 検出された問題
- 🟡 FINAL_MISSING×123 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×46  [2026-04-22T23:14:05]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×54  [2026-04-22T23:06:06]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×31  [2026-04-22T16:17:29]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-22T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.50+: n=6 pred=0.5304 actual=0.1667 gap=+0.3638`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-22T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.09MB / last modified 2026-04-23T02:00:02.037562+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
85 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-22 23:55:05,985 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-22 23:55:06,059 [INFO] predictor: Models loaded OK
2026-04-22 23:55:06,065 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-22 23:56:05,855 [INFO] run_cycle: === run_cycle 23:56:05 ===
2026-04-22 23:56:05,856 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-22 23:56:05,856 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-22 23:56:05,927 [INFO] predictor: Models loaded OK
2026-04-22 23:56:05,931 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-22 23:57:05,898 [INFO] run_cycle: === run_cycle 23:57:05 ===
2026-04-22 23:57:05,898 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-22 23:57:05,899 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-22 23:57:06,005 [INFO] predictor: Models loaded OK
2026-04-22 23:57:06,011 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-22 23:58:05,342 [INFO] run_cycle: === run_cycle 23:58:05 ===
2026-04-22 23:58:05,342 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-22 23:58:05,342 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-22 23:58:05,417 [INFO] predictor: Models loaded OK
2026-04-22 23:58:05,423 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-22 23:59:05,703 [INFO] run_cycle: === run_cycle 23:59:05 ===
2026-04-22 23:59:05,703 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-22 23:59:05,703 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-22 23:59:05,769 [INFO] predictor: Models loaded OK
2026-04-22 23:59:05,775 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 40
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 40
  }
]
```

## Phase別通知記録 (24h)
{'final': 12, 'result': 10, 'scan': 18}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 123
  ANOMALY_SCRAPER_FAILURE_BURST: 98
  ANOMALY_SCAN_FINAL_RATIO: 29
  ANOMALY_BET_VOLUME_SPIKE: 20
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 22 | 5 | 6,600 | 6,120 | -480 | 0.927 |

## 直近アラート (24h・新しい順)
```
[23:56:05] FINAL_MISSING: {"deadline": "2026-04-22T10:17:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042218051017", "sid": "S00"}
[23:40:08] FINAL_MISSING: {"deadline": "2026-04-22T13:03:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042222021303", "sid": "S00"}
[23:35:07] FINAL_MISSING: {"deadline": "2026-04-22T13:59:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042222041359", "sid": "S00"}
[23:35:07] FINAL_MISSING: {"deadline": "2026-04-22T11:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042206021158", "sid": "S00"}
[23:28:06] FINAL_MISSING: {"deadline": "2026-04-22T14:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042222061455", "sid": "S00"}
[23:28:06] FINAL_MISSING: {"deadline": "2026-04-22T11:51:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042218081151", "sid": "S00"}
[23:21:05] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.583, "baseline_mean": 0.917, "baseline_stdev": 0.144, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.333, "today_scan_count": 18, "z_score": -4.04}
[23:13:05] FINAL_MISSING: {"deadline": "2026-04-22T14:40:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042211091440", "sid": "S00"}
[23:13:05] FINAL_MISSING: {"deadline": "2026-04-22T11:34:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042211031134", "sid": "S00"}
[23:09:06] FINAL_MISSING: {"deadline": "2026-04-22T13:34:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042218111334", "sid": "S00"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 0件 登録 / 0件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 014R | win | 1 | 0.0156 | 45.3 | 0.71 | 300 | scan=- drift=- | 16:36:27 |
| S00 | 227R | win | 1 | 0.4111 | 4.6 | 1.89 | 300 | scan=- drift=- | 15:19:20 |
| S00 | 118R | win | 1 | 0.3177 | 8.1 | 2.57 | 300 | scan=25.5 drift=-68.2% | 14:05:45 |
| S00 | 066R | win | 1 | 0.5123 | 9.0 | 4.61 | 300 | scan=7.0 drift=+28.6% | 13:51:20 |
| S00 | 1810R | win | 1 | 0.4111 | 5.0 | 2.06 | 300 | scan=- drift=- | 12:55:44 |
| S00 | 115R | win | 1 | 0.0838 | 5.2 | 0.44 | 300 | scan=- drift=- | 12:27:21 |
| S00 | 063R | win | 1 | 0.5151 | 5.2 | 2.68 | 300 | scan=4.2 drift=+23.8% | 12:20:24 |
| S00 | 148R | win | 1 | 0.4111 | 6.4 | 2.63 | 300 | scan=4.8 drift=+33.3% | 11:59:27 |
| S00 | 114R | win | 1 | 0.4989 | 12.7 | 6.34 | 300 | scan=- drift=- | 11:58:45 |
| S00 | 111R | win | 1 | 0.5174 | 4.1 | 2.12 | 300 | scan=- drift=- | 10:34:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 9 | +6.1% | -68.2% | +33.3% | 2 | 1 | 8 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 406.5s |
| **Latency** (scan→final max) | 615.7s |
| **Traffic** (notifications 24h) | 40 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 22 | 0.4170 | 0.2273 | +0.1897 | 🟡+46% | 0.2060 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 22 | 0.4170 | 0.2273 | 0.2060 | 🔴-0.17 | 0.927 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 10 | 0.4187 | 0.3000 | 🔴+0.1187 |
| 0.50+ | 9 | 0.5253 | 0.2222 | 🔴+0.3030 |

## Settlement Ratio データ品質

- 学習済み: 0バンド / fallback: 16バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 1 | 0.35 |
| win | <10.0 | ⚠️fallback | 3 | 0.32 |
| win | <20.0 | ⚠️fallback | 1 | 0.22 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-04-23T02:10:01.927811+09:00_