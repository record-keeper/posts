# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-14T03:00:01.959698+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×88 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×51  [2026-10-13T23:09:05]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×20  [2026-10-13T15:41:33]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×46  [2026-10-13T13:05:20]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-10-13T11:15:22]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-13T11:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×18  [2026-10-13T10:00:39]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-13T06:00:25]
- key: `INSUFFICIENT_SAMPLE|S00: n=177<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-13T06:00:25]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=83<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-13T06:00:25]
- key: `ORPHAN_SCAN|164 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-13T06:00:25]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=168<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-10-13T06:00:25]
- key: `ROI_STAT|S00: n=177 hit%=24.3% hit_CI[Bonf]=[16.3,34.6]% ROI=0.67 ROI_boot95=[0.47,0.89]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-13T06:00:25]
- key: `ROI_STAT|S01_NAKAANA1: n=168 hit%=35.1% hit_CI[Bonf]=[25.4,46.2]% ROI=1.06 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-13T06:00:25]
- key: `ROI_STAT|S02_TETSUBAN: n=83 hit%=50.6% hit_CI[Bonf]=[35.4,65.7]% ROI=0.90 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-13T06:00:25]
- key: `DRIFT_BUCKET|drift ≤-30%: n=31 hit%=38.7% ROI=1.09 (コスト 9,000/回収 9,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-13T06:00:25]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=51 hit%=31.4% ROI=0.75 (コスト 12,100/回収 9,020)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-13T06:00:25]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=89 hit%=34.8% ROI=0.91 (コスト 20,400/回収 18,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-13T06:00:25]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=57 hit%=36.8% ROI=0.90 (コスト 13,400/回収 12,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-13T06:00:25]
- key: `DRIFT_BUCKET|drift ≥+30%: n=42 hit%=23.8% ROI=0.74 (コスト 10,900/回収 8,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-13T06:00:25]
- key: `CALIBRATION_LIVE|bt=win: n=428 pred=0.4819 actual=0.3364 error=+0.1454 (+30%) brier=0.2507 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-13T06:00:25]
- key: `CALIBRATION_LIVE|S00(win): n=177 pred=0.4515 hit=0.2429 cal_err=+0.2086 brier=0.2510 BSS=-0.36 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 15.73MB / last modified 2026-10-14T02:30:03.161171+09:00

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
61 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-13 23:55:04,261 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-13 23:55:04,307 [INFO] predictor: Models loaded OK
2026-10-13 23:55:04,311 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-13 23:56:04,281 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-10-13 23:56:04,281 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-13 23:56:04,281 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-13 23:56:04,330 [INFO] predictor: Models loaded OK
2026-10-13 23:56:04,334 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-13 23:57:04,391 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-10-13 23:57:04,391 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-13 23:57:04,391 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-13 23:57:04,444 [INFO] predictor: Models loaded OK
2026-10-13 23:57:04,447 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-13 23:58:04,145 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-10-13 23:58:04,145 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-13 23:58:04,145 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-13 23:58:04,195 [INFO] predictor: Models loaded OK
2026-10-13 23:58:04,197 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-13 23:59:04,011 [INFO] run_cycle: === run_cycle 23:59:04 ===
2026-10-13 23:59:04,011 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-13 23:59:04,011 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-13 23:59:04,047 [INFO] predictor: Models loaded OK
2026-10-13 23:59:04,050 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 64
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 64
  }
]
```

## Phase別通知記録 (24h)
{'final': 24, 'result': 15, 'scan': 25}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 109
  FINAL_MISSING: 88
  ANOMALY_SCAN_FINAL_RATIO: 18
  STRATEGY_CI_FAIL: 17
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 12 | 12,600 | 10,170 | -2,430 | 0.807 |
| S01_NAKAANA1 | 35 | 14 | 7,000 | 6,280 | -720 | 0.897 |
| S02_TETSUBAN | 21 | 10 | 4,200 | 4,040 | -160 | 0.962 |

## 直近アラート (24h・新しい順)
```
[23:54:03] FINAL_MISSING: {"deadline": "2026-10-13T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101311031116", "sid": "S01_NAKAANA1"}
[23:54:03] FINAL_MISSING: {"deadline": "2026-10-13T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101311031116", "sid": "S00"}
[23:53:04] FINAL_MISSING: {"deadline": "2026-10-13T17:17:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101320051717", "sid": "S00"}
[23:48:04] FINAL_MISSING: {"deadline": "2026-10-13T14:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101322071414", "sid": "S00"}
[23:30:10] FINAL_MISSING: {"deadline": "2026-10-13T10:52:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101314061052", "sid": "S01_NAKAANA1"}
[23:30:10] FINAL_MISSING: {"deadline": "2026-10-13T10:52:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101314061052", "sid": "S00"}
[23:28:04] FINAL_MISSING: {"deadline": "2026-10-13T17:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101312071755", "sid": "S00"}
[23:27:05] FINAL_MISSING: {"deadline": "2026-10-13T10:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101311021050", "sid": "S01_NAKAANA1"}
[23:09:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[22:53:04] FINAL_MISSING: {"deadline": "2026-10-13T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101311031116", "sid": "S01_NAKAANA1"}
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
| S00 | 194R | win | 1 | 0.1720 | 15.2 | 2.61 | 300 | scan=- drift=- | 19:00:32 |
| S00 | 204R | win | 1 | 0.4111 | 6.6 | 2.71 | 300 | scan=4.3 drift=+53.5% | 16:49:18 |
| S00 | 153R | win | 1 | 0.4989 | 8.2 | 4.09 | 300 | scan=12.7 drift=-35.4% | 16:12:19 |
| S00 | 229R | win | 1 | 0.5174 | 6.9 | 3.57 | 300 | scan=- drift=- | 15:07:30 |
| S02_TETSUBAN | 119R | win | 1 | 0.5174 | 2.3 | 1.19 | 200 | scan=2.1 drift=+9.5% | 14:18:20 |
| S02_TETSUBAN | 138R | win | 1 | 0.5334 | 2.4 | 1.28 | 200 | scan=2.4 drift=+0.0% | 14:05:20 |
| S01_NAKAANA1 | 067R | win | 1 | 0.4111 | 3.2 | 1.32 | 200 | scan=- drift=- | 13:43:20 |
| S00 | 224R | win | 1 | 0.5123 | 18.7 | 9.58 | 300 | scan=17.2 drift=+8.7% | 12:36:18 |
| S00 | 064R | win | 1 | 0.5123 | 11.2 | 5.74 | 300 | scan=9.7 drift=+15.5% | 12:14:31 |
| S01_NAKAANA1 | 223R | win | 1 | 0.5735 | 4.1 | 2.35 | 200 | scan=- drift=- | 12:11:23 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 59 | +14.0% | -60.0% | +326.7% | 16 | 7 | 41 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 516.7s |
| **Latency** (scan→final max) | 634.2s |
| **Traffic** (notifications 24h) | 64 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 428 | 0.4816 | 0.3411 | +0.1405 | 🟡+29% | 0.2488 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 180 | 0.4504 | 0.2556 | 0.2487 | 🔴-0.31 | 0.689 |
| S01_NAKAANA1 | win | 166 | 0.4924 | 0.3494 | 0.2443 | 🔴-0.07 | 1.034 |
| S02_TETSUBAN | win | 82 | 0.5280 | 0.5122 | 0.2584 | 🔴-0.03 | 0.934 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.20-0.30 | 5 | 0.2245 | 0.2000 | ✅+0.0245 |
| 0.30-0.50 | 154 | 0.4178 | 0.2987 | 🔴+0.1191 |
| 0.50+ | 256 | 0.5435 | 0.3711 | 🔴+0.1724 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 180 | 0.775 |
| win | <5.0 | ✅learned | 321 | 0.753 |
| win | <10.0 | ✅learned | 139 | 0.46 |
| win | <20.0 | ✅learned | 41 | 0.24 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-10-14T03:00:01.959698+09:00_