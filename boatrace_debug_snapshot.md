# ClaudeDebug スナップショット

## 🟡 現状: YELLOW

**生成**: 2026-04-28T16:50:01.494047+09:00

### 次に取るべきアクション
> YELLOW監視: FINAL_MISSING×42 (24h)

### 検出された問題
- 🟡 FINAL_MISSING×42 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×23  [2026-04-28T16:27:06]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-04-28T16:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×17  [2026-04-28T11:01:31]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ ROI_STAT  ×1  [2026-04-28T06:00:07]
- key: `ROI_STAT|S00: n=61 hit%=23.0% hit_CI[Bonf]=[11.3,41.1]% ROI=0.82 ROI_boot95=[0.40,1.26]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-04-28T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=61<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-04-28T06:00:07]
- key: `ORPHAN_SCAN|51 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-28T06:00:07]
- key: `CALIBRATION_LIVE|bt=win: n=61 pred=0.4398 actual=0.2295 error=+0.2103 (+48%) brier=0.2299 [OVERCO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-28T06:00:07]
- key: `CALIBRATION_LIVE|S00(win): n=61 pred=0.4398 hit=0.2295 cal_err=+0.2103 brier=0.2299 BSS=-0.30 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-28T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=26 pred=0.4462 actual=0.2308 gap=+0.2154`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-28T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.50+: n=25 pred=0.5328 actual=0.2800 gap=+0.2528`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-28T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-28T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=881 bet=300 odds=12.7 payout=900 ratio=0.24`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-28T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=906 bet=300 odds=14.2 payout=360 ratio=0.08`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-28T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=913 bet=300 odds=4.6 payout=2550 ratio=1.85`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-28T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=917 bet=300 odds=6.2 payout=390 ratio=0.21`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.34MB / last modified 2026-04-28T16:49:05.749700+09:00

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
 run_cycle 16:48:05 ===
2026-04-28 16:48:05,636 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-28 16:48:05,636 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-28 16:48:05,705 [INFO] predictor: Models loaded OK
2026-04-28 16:48:17,200 [INFO] scraper: odds3t: 120/120 parsed
2026-04-28 16:48:18,308 [INFO] scraper: odds3f: 20/20 parsed
2026-04-28 16:48:19,400 [INFO] scraper: odds2t: 30/30 parsed
2026-04-28 16:48:19,401 [INFO] scraper: odds2f: 15/15 parsed
2026-04-28 16:48:20,477 [INFO] scraper: odds_win: 6/6 parsed
2026-04-28 16:48:20,477 [INFO] scraper: fetch_race 16/12: boats=6 odds=191/191
2026-04-28 16:48:20,490 [INFO] predictor: CALIBRATION_MODE=on
2026-04-28 16:48:20,490 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-04-28 16:48:20,498 [INFO] run_cycle: fetched 16/12 [final]: 156 combos
2026-04-28 16:48:24,004 [INFO] scraper: odds3t: 120/120 parsed
2026-04-28 16:48:25,165 [INFO] scraper: odds3f: 20/20 parsed
2026-04-28 16:48:26,402 [INFO] scraper: odds2t: 28/30 parsed
2026-04-28 16:48:26,403 [INFO] scraper: odds2f: 13/15 parsed
2026-04-28 16:48:27,488 [INFO] scraper: odds_win: 2/6 parsed
2026-04-28 16:48:27,490 [INFO] scraper: fetch_race 07/5: boats=6 odds=183/191
2026-04-28 16:48:27,504 [INFO] predictor: CALIBRATION_MODE=on
2026-04-28 16:48:27,508 [INFO] predictor: combos: {'win': 2, '2t': 28, '3t': 120}
2026-04-28 16:48:27,516 [INFO] run_cycle: fetched 07/5 [scan]: 150 combos
2026-04-28 16:48:27,646 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-28 16:49:05,573 [INFO] run_cycle: === run_cycle 16:49:05 ===
2026-04-28 16:49:05,573 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-28 16:49:05,573 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-28 16:49:05,618 [INFO] predictor: Models loaded OK
2026-04-28 16:49:05,700 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 48
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 48
  }
]
```

## Phase別通知記録 (24h)
{'final': 20, 'result': 6, 'scan': 22}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 180
  FINAL_MISSING: 42
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 53 | 13 | 15,900 | 12,270 | -3,630 | 0.772 |

## 直近アラート (24h・新しい順)
```
[16:48:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1046}
[16:47:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1043}
[16:46:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1051}
[16:45:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1062}
[16:43:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1072}
[16:42:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1065}
[16:41:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1069}
[16:40:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1068}
[16:39:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1052}
[16:38:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1068}
```

## 本日残レース: 39件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 129件 締切済
- 通知発射: scan=14 nid / final=13 nid / result=4 nid
- predictions: 4 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 152R | win | 1 | 0.4989 | 12.7 | 6.34 | 300 | scan=12.7 drift=+0.0% | 15:48:20 |
| S00 | 087R | win | 1 | 0.5891 | 5.9 | 3.48 | 300 | scan=9.0 drift=-34.4% | 13:08:32 |
| S00 | 162R | win | 1 | 0.3177 | 7.2 | 2.29 | 300 | scan=6.4 drift=+12.5% | 11:19:32 |
| S00 | 186R | win | 1 | 0.5002 | 4.5 | 2.25 | 300 | scan=- drift=- | 10:54:20 |
| S00 | 245R | win | 1 | 0.3177 | 4.6 | 1.46 | 300 | scan=4.0 drift=+15.0% | 19:27:20 |
| S00 | 155R | win | 1 | 0.4111 | 15.7 | 6.45 | 300 | scan=16.5 drift=-4.8% | 17:16:22 |
| S00 | 063R | win | 1 | 0.4111 | 5.0 | 2.06 | 300 | scan=13.5 drift=-63.0% | 12:28:20 |
| S00 | 085R | win | 1 | 0.4989 | 5.5 | 2.74 | 300 | scan=7.1 drift=-22.5% | 12:12:32 |
| S00 | 188R | win | 1 | 0.5334 | 4.2 | 2.24 | 300 | scan=8.2 drift=-48.8% | 11:57:19 |
| S00 | 043R | win | 1 | 0.4989 | 18.7 | 9.33 | 300 | scan=- drift=- | 11:50:49 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 33 | +7.0% | -68.2% | +156.7% | 15 | 9 | 27 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 448.3s |
| **Latency** (scan→final max) | 616.6s |
| **Traffic** (notifications 24h) | 48 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 65 | 0.4421 | 0.2308 | +0.2113 | 🟡+48% | 0.2276 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 65 | 0.4421 | 0.2308 | 0.2276 | 🔴-0.28 | 0.789 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 31 | 0.4326 | 0.1935 | 🔴+0.2390 |
| 0.50+ | 27 | 0.5337 | 0.2963 | 🔴+0.2374 |

## Settlement Ratio データ品質

- 学習済み: 0バンド / fallback: 16バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 4 | 0.35 |
| win | <10.0 | ⚠️fallback | 9 | 0.32 |
| win | <20.0 | ⚠️fallback | 2 | 0.22 |
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
_auto-generated by claude_snapshot.py at 2026-04-28T16:50:01.494047+09:00_