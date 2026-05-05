# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-05T12:10:02.120559+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×30 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×51 (24h)
- 🔴 PSI_DRIFT_DETECTED×30 (24h)
- 🔴 CALIBRATION_DRIFT×28 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CALIBRATION_DRIFT  ×7  [2026-05-05T12:03:20]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×7  [2026-05-05T12:03:20]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×7  [2026-05-05T12:03:20]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×8  [2026-05-05T12:02:26]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-05-05T11:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_DROP  ×59  [2026-05-05T10:00:26]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-05T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=7 pred=0.2227 actual=0.2857 gap=-0.0630`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-05T06:00:07]
- key: `ROI_STAT|S00: n=110 hit%=20.9% hit_CI[Bonf]=[12.0,33.9]% ROI=0.80 ROI_boot95=[0.49,1.17]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-05T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=110<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-05T06:00:07]
- key: `ORPHAN_SCAN|95 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-05T06:00:07]
- key: `CALIBRATION_LIVE|bt=win: n=110 pred=0.4298 actual=0.2091 error=+0.2207 (+51%) brier=0.2298 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🔴 CALIBRATION_DRIFT  ×1  [2026-05-05T06:00:07]
- key: `CALIBRATION_DRIFT|bt=win: pred=0.4298 actual=0.2091 (+51% overconfident, n=110). EV = p * odds is `
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-05T06:00:07]
- key: `CALIBRATION_LIVE|S00(win): n=110 pred=0.4298 hit=0.2091 cal_err=+0.2207 brier=0.2298 BSS=-0.39 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-05T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=10 pred=0.3276 actual=0.1000 gap=+0.2276`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-05T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=44 pred=0.4438 actual=0.2045 gap=+0.2393`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-05T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.50+: n=41 pred=0.5327 actual=0.2195 gap=+0.3132`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-05T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-05T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=881 bet=300 odds=12.7 payout=900 ratio=0.24`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-05T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=906 bet=300 odds=14.2 payout=360 ratio=0.08`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-05T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=913 bet=300 odds=4.6 payout=2550 ratio=1.85`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.83MB / last modified 2026-05-05T12:09:28.578962+09:00

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
rsed
2026-05-05 12:08:20,785 [INFO] scraper: fetch_race 09/5: boats=6 odds=183/191
2026-05-05 12:08:20,805 [INFO] predictor: CALIBRATION_MODE=on
2026-05-05 12:08:20,805 [INFO] predictor: combos: {'win': 2, '2t': 30, '3t': 120}
2026-05-05 12:08:20,812 [INFO] run_cycle: fetched 09/5 [scan]: 152 combos
2026-05-05 12:08:20,926 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-05 12:09:06,044 [INFO] run_cycle: === run_cycle 12:09:06 ===
2026-05-05 12:09:06,044 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-05 12:09:06,044 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-05 12:09:06,121 [INFO] predictor: Models loaded OK
2026-05-05 12:09:17,640 [INFO] scraper: odds3t: 120/120 parsed
2026-05-05 12:09:18,741 [INFO] scraper: odds3f: 19/20 parsed
2026-05-05 12:09:19,848 [INFO] scraper: odds2t: 30/30 parsed
2026-05-05 12:09:19,850 [INFO] scraper: odds2f: 15/15 parsed
2026-05-05 12:09:20,935 [INFO] scraper: odds_win: 5/6 parsed
2026-05-05 12:09:20,935 [INFO] scraper: fetch_race 17/4: boats=6 odds=189/191
2026-05-05 12:09:20,947 [INFO] predictor: CALIBRATION_MODE=on
2026-05-05 12:09:20,947 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-05-05 12:09:20,955 [INFO] run_cycle: fetched 17/4 [final]: 155 combos
2026-05-05 12:09:25,053 [INFO] scraper: odds3t: 120/120 parsed
2026-05-05 12:09:26,130 [INFO] scraper: odds3f: 20/20 parsed
2026-05-05 12:09:27,254 [INFO] scraper: odds2t: 26/30 parsed
2026-05-05 12:09:27,255 [INFO] scraper: odds2f: 15/15 parsed
2026-05-05 12:09:28,387 [INFO] scraper: odds_win: 6/6 parsed
2026-05-05 12:09:28,387 [INFO] scraper: fetch_race 13/5: boats=6 odds=187/191
2026-05-05 12:09:28,396 [INFO] predictor: CALIBRATION_MODE=on
2026-05-05 12:09:28,396 [INFO] predictor: combos: {'win': 6, '2t': 26, '3t': 120}
2026-05-05 12:09:28,409 [INFO] run_cycle: fetched 13/5 [scan]: 152 combos
2026-05-05 12:09:28,552 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 41
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 41
  }
]
```

## Phase別通知記録 (24h)
{'final': 16, 'result': 10, 'scan': 15}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 210
  FINAL_MISSING: 51
  PSI_DRIFT_DETECTED: 30
  CALIBRATION_DRIFT: 28
  CIRCUIT_BREAKER_NO_ACTION: 17
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 53 | 10 | 15,900 | 12,210 | -3,690 | 0.768 |

## 直近アラート (24h・新しい順)
```
[12:09:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1368}
[12:07:53] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1350}
[12:06:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1388}
[12:05:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1384}
[12:04:28] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 63, "n_recent": 53, "psi": 0.838}
[12:04:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1374}
[12:03:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[12:03:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1367}
[12:02:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1385}
[12:01:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1372}
```

## 本日残レース: 152件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 204件 登録 / 52件 締切済
- 通知発射: scan=11 nid / final=10 nid / result=3 nid
- predictions: 6 / うち結果DB記録済: 3
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 108R | win | 1 | 0.2290 | 10.3 | 2.36 | 300 | scan=10.2 drift=+1.0% | 12:04:20 |
| S00 | 163R | win | 1 | 0.5174 | 6.0 | 3.10 | 300 | scan=7.0 drift=-14.3% | 12:00:24 |
| S00 | 062R | win | 1 | 0.4111 | 5.5 | 2.26 | 300 | scan=7.6 drift=-27.6% | 11:55:31 |
| S00 | 133R | win | 1 | 0.3995 | 21.7 | 8.67 | 300 | scan=- drift=- | 11:23:27 |
| S00 | 106R | win | 1 | 0.4111 | 13.5 | 5.55 | 300 | scan=31.5 drift=-57.1% | 11:02:33 |
| S00 | 234R | win | 1 | 0.5891 | 12.5 | 7.36 | 300 | scan=13.8 drift=-9.4% | 09:47:20 |
| S00 | 073R | win | 1 | 0.3783 | 7.6 | 2.88 | 300 | scan=9.5 drift=-20.0% | 16:18:21 |
| S00 | 011R | win | 1 | 0.4111 | 13.9 | 5.71 | 300 | scan=- drift=- | 15:15:41 |
| S00 | 166R | win | 1 | 0.5174 | 42.7 | 22.09 | 300 | scan=- drift=- | 13:27:21 |
| S00 | 1010R | win | 1 | 0.4111 | 6.1 | 2.51 | 300 | scan=4.5 drift=+35.6% | 13:02:29 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 37 | -5.8% | -81.4% | +117.3% | 16 | 10 | 26 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 459.6s |
| **Latency** (scan→final max) | 599.4s |
| **Traffic** (notifications 24h) | 41 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 113 | 0.4308 | 0.2124 | +0.2184 | 🔴+51% | 0.2281 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 113 | 0.4308 | 0.2124 | 0.2281 | 🔴-0.36 | 0.801 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.20-0.30 | 7 | 0.2227 | 0.2857 | 🔴-0.0630 |
| 0.30-0.50 | 56 | 0.4217 | 0.1786 | 🔴+0.2431 |
| 0.50+ | 42 | 0.5341 | 0.2381 | 🔴+0.2960 |

## Settlement Ratio データ品質

- 学習済み: 1バンド / fallback: 15バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 5 | 0.35 |
| win | <10.0 | ✅learned | 16 | 0.61 |
| win | <20.0 | ⚠️fallback | 3 | 0.22 |
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
_auto-generated by claude_snapshot.py at 2026-05-05T12:10:02.120559+09:00_