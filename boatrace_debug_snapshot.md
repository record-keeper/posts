# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-23T09:40:01.477420+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×24 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×39  [2026-05-23T09:01:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×39  [2026-05-23T09:01:06]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ORPHAN_SCAN  ×1  [2026-05-23T06:00:10]
- key: `ORPHAN_SCAN|240 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-23T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=5 pred=0.1288 actual=0.2000 gap=-0.0712`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-23T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1957 actual=0.1667 gap=+0.0291`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-23T06:00:10]
- key: `ROI_STAT|S00: n=196 hit%=28.6% hit_CI[Bonf]=[20.3,38.6]% ROI=0.96 ROI_boot95=[0.71,1.24]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-23T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=196<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-23T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=65 hit%=32.3% hit_CI[Bonf]=[18.4,50.2]% ROI=0.85 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-23T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=65<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-23T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=40 hit%=45.0% hit_CI[Bonf]=[25.2,66.5]% ROI=0.83 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-23T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=40<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-23T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=50 hit%=32.0% ROI=0.86 (コスト 14,800/回収 12,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-23T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=39 hit%=30.8% ROI=1.28 (コスト 9,300/回収 11,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-23T06:00:10]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=59 hit%=27.1% ROI=0.92 (コスト 14,400/回収 13,200)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-23T06:00:10]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=23 hit%=34.8% ROI=1.31 (コスト 5,700/回収 7,470)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-23T06:00:10]
- key: `DRIFT_BUCKET|drift ≥+30%: n=38 hit%=18.4% ROI=0.51 (コスト 10,000/回収 5,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-23T06:00:10]
- key: `CALIBRATION_LIVE|bt=win: n=301 pred=0.4570 actual=0.3156 error=+0.1414 (+31%) brier=0.2332 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-23T06:00:10]
- key: `CALIBRATION_LIVE|S00(win): n=196 pred=0.4369 hit=0.2857 cal_err=+0.1512 brier=0.2267 BSS=-0.11 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-23T06:00:10]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=65 pred=0.4832 hit=0.3231 cal_err=+0.1602 brier=0.2405 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-23T06:00:10]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=40 pred=0.5126 hit=0.4500 cal_err=+0.0626 brier=0.2529 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.2MB / last modified 2026-05-23T09:39:05.827393+09:00

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
[INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-23 09:37:06,698 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-23 09:37:06,785 [INFO] predictor: Models loaded OK
2026-05-23 09:37:17,845 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=4&jcd=23&hd=20260523: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-05-23 09:37:29,236 [INFO] scraper: odds3t: 120/120 parsed
2026-05-23 09:37:30,308 [INFO] scraper: odds3f: 20/20 parsed
2026-05-23 09:37:31,470 [INFO] scraper: odds2t: 29/30 parsed
2026-05-23 09:37:31,472 [INFO] scraper: odds2f: 15/15 parsed
2026-05-23 09:37:32,774 [INFO] scraper: odds_win: 6/6 parsed
2026-05-23 09:37:32,774 [INFO] scraper: fetch_race 23/4: boats=6 odds=190/191
2026-05-23 09:37:32,785 [INFO] predictor: CALIBRATION_MODE=on
2026-05-23 09:37:32,785 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-05-23 09:37:32,791 [INFO] run_cycle: fetched 23/4 [scan]: 155 combos
2026-05-23 09:37:32,891 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-23 09:38:05,333 [INFO] run_cycle: === run_cycle 09:38:05 ===
2026-05-23 09:38:05,333 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-23 09:38:05,333 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-23 09:38:05,402 [INFO] predictor: Models loaded OK
2026-05-23 09:38:05,526 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-23 09:39:05,512 [INFO] run_cycle: === run_cycle 09:39:05 ===
2026-05-23 09:39:05,514 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-23 09:39:05,514 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-23 09:39:05,584 [INFO] predictor: Models loaded OK
2026-05-23 09:39:05,775 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 61
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 61
  }
]
```

## Phase別通知記録 (24h)
{'final': 24, 'result': 17, 'scan': 20}

## アラート件数 (24h・種類別)
```
  KS_ODDS_DRIFT: 41
  ANOMALY_SCRAPER_FAILURE_BURST: 29
  FINAL_MISSING: 24
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 10
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 31 | 13 | 9,300 | 14,880 | +5,580 | 1.6 |
| S01_NAKAANA1 | 27 | 7 | 5,400 | 5,420 | +20 | 1.004 |
| S02_TETSUBAN | 13 | 5 | 2,600 | 1,640 | -960 | 0.631 |

## 直近アラート (24h・新しい順)
```
[09:08:05] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.003138, "ks_stat": 0.24}
[09:01:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:01:05] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.001736, "ks_stat": 0.249}
[08:00:35] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:00:35] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.001736, "ks_stat": 0.249}
[06:00:07] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:07] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.001736, "ks_stat": 0.249}
[23:58:06] FINAL_MISSING: {"deadline": "2026-05-22T17:26:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052201051726", "sid": "S00"}
[23:24:05] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.001736, "ks_stat": 0.249}
[23:16:06] FINAL_MISSING: {"deadline": "2026-05-22T18:44:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052201081844", "sid": "S00"}
```

## 本日残レース: 147件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 9件 締切済
- 通知発射: scan=1 nid / final=1 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 197R | win | 1 | 0.5998 | 3.4 | 2.04 | 200 | scan=3.5 drift=-2.9% | 20:22:22 |
| S00 | 019R | win | 1 | 0.4111 | 5.2 | 2.14 | 300 | scan=11.0 drift=-52.7% | 19:10:35 |
| S01_NAKAANA1 | 015R | win | 1 | 0.4111 | 4.2 | 1.73 | 200 | scan=3.2 drift=+31.2% | 17:23:45 |
| S01_NAKAANA1 | 014R | win | 1 | 0.5123 | 3.4 | 1.74 | 200 | scan=- drift=- | 16:59:33 |
| S01_NAKAANA1 | 013R | win | 1 | 0.3177 | 3.1 | 0.98 | 200 | scan=- drift=- | 16:25:21 |
| S01_NAKAANA1 | 152R | win | 1 | 0.5123 | 4.5 | 2.31 | 200 | scan=3.7 drift=+21.6% | 16:04:21 |
| S00 | 011R | win | 1 | 0.3177 | 4.6 | 1.46 | 300 | scan=18.3 drift=-74.9% | 15:22:45 |
| S01_NAKAANA1 | 055R | win | 1 | 0.4111 | 4.2 | 1.73 | 200 | scan=- drift=- | 13:42:21 |
| S00 | 097R | win | 1 | 0.4111 | 6.7 | 2.75 | 300 | scan=5.6 drift=+19.6% | 13:21:32 |
| S00 | 087R | win | 1 | 0.4111 | 5.0 | 2.06 | 300 | scan=- drift=- | 13:10:24 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 40 | +2.6% | -74.9% | +148.9% | 15 | 8 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 443.1s |
| **Latency** (scan→final max) | 617.8s |
| **Traffic** (notifications 24h) | 61 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 301 | 0.4570 | 0.3156 | +0.1414 | 🟡+31% | 0.2332 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 196 | 0.4369 | 0.2857 | 0.2267 | 🔴-0.11 | 0.959 |
| S01_NAKAANA1 | win | 65 | 0.4832 | 0.3231 | 0.2405 | 🔴-0.10 | 0.849 |
| S02_TETSUBAN | win | 40 | 0.5126 | 0.4500 | 0.2529 | 🔴-0.02 | 0.83 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 13 | 0.0041 | 0.0769 | 🔴-0.0729 |
| 0.10-0.15 | 5 | 0.1288 | 0.2000 | 🔴-0.0712 |
| 0.15-0.20 | 6 | 0.1957 | 0.1667 | ✅+0.0291 |
| 0.20-0.30 | 12 | 0.2243 | 0.3333 | 🔴-0.1090 |
| 0.30-0.50 | 134 | 0.4198 | 0.2463 | 🔴+0.1736 |
| 0.50+ | 142 | 0.5398 | 0.3944 | 🔴+0.1455 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 18 | 0.755 |
| win | <5.0 | ✅learned | 37 | 0.806 |
| win | <10.0 | ✅learned | 33 | 0.545 |
| win | <20.0 | ✅learned | 11 | 0.193 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-05-23T09:40:01.477420+09:00_